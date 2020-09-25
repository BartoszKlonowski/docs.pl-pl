---
title: RZUTowanie (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 07b6d750-dfd4-48a9-b86c-3badcbba6f70
ms.openlocfilehash: 5591f1947963dde45d34ad2342485af476765709
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91198018"
---
# <a name="cast-entity-sql"></a><span data-ttu-id="c34f8-102">RZUTowanie (Entity SQL)</span><span class="sxs-lookup"><span data-stu-id="c34f8-102">CAST (Entity SQL)</span></span>

<span data-ttu-id="c34f8-103">Konwertuje wyrażenie jednego typu danych na inne.</span><span class="sxs-lookup"><span data-stu-id="c34f8-103">Converts an expression of one data type to another.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c34f8-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="c34f8-104">Syntax</span></span>  
  
```csharp
CAST ( expression AS data_type )  
```  
  
## <a name="arguments"></a><span data-ttu-id="c34f8-105">Argumenty</span><span class="sxs-lookup"><span data-stu-id="c34f8-105">Arguments</span></span>  

 `expression`  
 <span data-ttu-id="c34f8-106">Dowolne prawidłowe wyrażenie, które jest konwertowane na `data_type` .</span><span class="sxs-lookup"><span data-stu-id="c34f8-106">Any valid expression that is convertible to `data_type`.</span></span>  
  
 `data_type`  
 <span data-ttu-id="c34f8-107">Docelowy typ danych dostarczany przez system.</span><span class="sxs-lookup"><span data-stu-id="c34f8-107">The target system-supplied data type.</span></span> <span data-ttu-id="c34f8-108">Musi to być typ pierwotny (skalarny).</span><span class="sxs-lookup"><span data-stu-id="c34f8-108">It must be a primitive (scalar) type.</span></span> <span data-ttu-id="c34f8-109">`data_type`Użycie zależy od przestrzeni zapytania.</span><span class="sxs-lookup"><span data-stu-id="c34f8-109">The `data_type` used depends on the query space.</span></span> <span data-ttu-id="c34f8-110">Jeśli zapytanie jest wykonywane z <xref:System.Data.EntityClient.EntityCommand> , typ danych jest typem zdefiniowanym w modelu koncepcyjnym.</span><span class="sxs-lookup"><span data-stu-id="c34f8-110">If a query is executed with the <xref:System.Data.EntityClient.EntityCommand>, the data type is a type defined in the conceptual model.</span></span> <span data-ttu-id="c34f8-111">Aby uzyskać więcej informacji, zobacz [Specyfikacja CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec).</span><span class="sxs-lookup"><span data-stu-id="c34f8-111">For more information, see [CSDL Specification](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec).</span></span> <span data-ttu-id="c34f8-112">Jeśli zapytanie jest wykonywane z <xref:System.Data.Objects.ObjectQuery%601> , typem danych jest typ środowiska uruchomieniowego języka wspólnego (CLR).</span><span class="sxs-lookup"><span data-stu-id="c34f8-112">If a query is executed with <xref:System.Data.Objects.ObjectQuery%601>, the data type is a common language runtime (CLR) type.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="c34f8-113">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="c34f8-113">Return Value</span></span>  

 <span data-ttu-id="c34f8-114">Zwraca tę samą wartość, co `data_type` .</span><span class="sxs-lookup"><span data-stu-id="c34f8-114">Returns the same value as `data_type`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="c34f8-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c34f8-115">Remarks</span></span>  

 <span data-ttu-id="c34f8-116">Wyrażenie cast ma podobną semantykę wyrażenia konwersji Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="c34f8-116">The cast expression has similar semantics to the Transact-SQL CONVERT expression.</span></span> <span data-ttu-id="c34f8-117">Wyrażenie cast służy do konwertowania wartości jednego typu na wartość innego typu.</span><span class="sxs-lookup"><span data-stu-id="c34f8-117">The cast expression is used to convert a value of one type into a value of another type.</span></span>  
  
```csharp
CAST( e as T )  
```  
  
 <span data-ttu-id="c34f8-118">Jeśli e jest typu S, a S jest konwertowany na T, powyższe wyrażenie jest prawidłowym wyrażeniem rzutowania.</span><span class="sxs-lookup"><span data-stu-id="c34f8-118">If e is of some type S, and S is convertible to T, then the above expression is a valid cast expression.</span></span> <span data-ttu-id="c34f8-119">T musi być typem pierwotnym (skalarnym).</span><span class="sxs-lookup"><span data-stu-id="c34f8-119">T must be a primitive (scalar) type.</span></span>  
  
 <span data-ttu-id="c34f8-120">Wartości dla aspektów dokładności i skalowania mogą opcjonalnie być podane podczas rzutowania do `Edm.Decimal` .</span><span class="sxs-lookup"><span data-stu-id="c34f8-120">Values for the precision and scale facets may optionally be provided when casting to `Edm.Decimal`.</span></span> <span data-ttu-id="c34f8-121">Jeśli nie podano ich jawnie, domyślne wartości dokładności i skali są odpowiednio 18 i 0.</span><span class="sxs-lookup"><span data-stu-id="c34f8-121">If not explicitly provided, the default values for precision and scale are 18 and 0, respectively.</span></span> <span data-ttu-id="c34f8-122">W szczególnych przypadkach obsługiwane są następujące przeciążenia `Decimal` :</span><span class="sxs-lookup"><span data-stu-id="c34f8-122">Specifically, the following overloads are supported for `Decimal`:</span></span>  
  
- `CAST( d as Edm.Decimal );`  
  
- `CAST( d as Edm.Decimal(precision) );`  
  
- `CAST( d as Edm.Decimal(precision, scale) );`  
  
 <span data-ttu-id="c34f8-123">Użycie wyrażenia Cast jest uznawane za jawną konwersję.</span><span class="sxs-lookup"><span data-stu-id="c34f8-123">The use of a cast expression is considered an explicit conversion.</span></span> <span data-ttu-id="c34f8-124">Konwersje jawne mogą obciąć dane lub utracić precyzję.</span><span class="sxs-lookup"><span data-stu-id="c34f8-124">Explicit conversions might truncate data or lose precision.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="c34f8-125">RZUTowanie jest obsługiwane tylko dla typów pierwotnych i typów elementów członkowskich wyliczenia.</span><span class="sxs-lookup"><span data-stu-id="c34f8-125">CAST is only supported over primitive types and enumeration member types.</span></span>  
  
## <a name="example"></a><span data-ttu-id="c34f8-126">Przykład</span><span class="sxs-lookup"><span data-stu-id="c34f8-126">Example</span></span>  

 <span data-ttu-id="c34f8-127">Następujące [!INCLUDE[esql](../../../../../../includes/esql-md.md)] zapytanie używa operatora Cast do rzutowania wyrażenia jednego typu danych na inny.</span><span class="sxs-lookup"><span data-stu-id="c34f8-127">The following [!INCLUDE[esql](../../../../../../includes/esql-md.md)] query uses the CAST operator to cast an expression of one data type to another.</span></span> <span data-ttu-id="c34f8-128">Zapytanie jest oparte na modelu sprzedaży AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="c34f8-128">The query is based on the AdventureWorks Sales Model.</span></span> <span data-ttu-id="c34f8-129">Aby skompilować i uruchomić to zapytanie, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c34f8-129">To compile and run this query, follow these steps:</span></span>  
  
1. <span data-ttu-id="c34f8-130">Postępuj zgodnie z procedurą w [instrukcje: wykonywanie zapytania, które zwraca wyniki typu pierwotnego](../how-to-execute-a-query-that-returns-primitivetype-results.md).</span><span class="sxs-lookup"><span data-stu-id="c34f8-130">Follow the procedure in [How to: Execute a Query that Returns PrimitiveType Results](../how-to-execute-a-query-that-returns-primitivetype-results.md).</span></span>  
  
2. <span data-ttu-id="c34f8-131">Przekaż następujące zapytanie jako argument do `ExecutePrimitiveTypeQuery` metody:</span><span class="sxs-lookup"><span data-stu-id="c34f8-131">Pass the following query as an argument to the `ExecutePrimitiveTypeQuery` method:</span></span>  
  
 [!code-csharp[DP EntityServices Concepts 2#CAST](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#cast)]  
  
## <a name="see-also"></a><span data-ttu-id="c34f8-132">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c34f8-132">See also</span></span>

- [<span data-ttu-id="c34f8-133">Odwołanie do jednostki SQL</span><span class="sxs-lookup"><span data-stu-id="c34f8-133">Entity SQL Reference</span></span>](entity-sql-reference.md)
