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
# <a name="cast-entity-sql"></a>RZUTowanie (Entity SQL)

Konwertuje wyrażenie jednego typu danych na inne.  
  
## <a name="syntax"></a>Składnia  
  
```csharp
CAST ( expression AS data_type )  
```  
  
## <a name="arguments"></a>Argumenty  

 `expression`  
 Dowolne prawidłowe wyrażenie, które jest konwertowane na `data_type` .  
  
 `data_type`  
 Docelowy typ danych dostarczany przez system. Musi to być typ pierwotny (skalarny). `data_type`Użycie zależy od przestrzeni zapytania. Jeśli zapytanie jest wykonywane z <xref:System.Data.EntityClient.EntityCommand> , typ danych jest typem zdefiniowanym w modelu koncepcyjnym. Aby uzyskać więcej informacji, zobacz [Specyfikacja CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec). Jeśli zapytanie jest wykonywane z <xref:System.Data.Objects.ObjectQuery%601> , typem danych jest typ środowiska uruchomieniowego języka wspólnego (CLR).  
  
## <a name="return-value"></a>Wartość zwracana  

 Zwraca tę samą wartość, co `data_type` .  
  
## <a name="remarks"></a>Uwagi  

 Wyrażenie cast ma podobną semantykę wyrażenia konwersji Transact-SQL. Wyrażenie cast służy do konwertowania wartości jednego typu na wartość innego typu.  
  
```csharp
CAST( e as T )  
```  
  
 Jeśli e jest typu S, a S jest konwertowany na T, powyższe wyrażenie jest prawidłowym wyrażeniem rzutowania. T musi być typem pierwotnym (skalarnym).  
  
 Wartości dla aspektów dokładności i skalowania mogą opcjonalnie być podane podczas rzutowania do `Edm.Decimal` . Jeśli nie podano ich jawnie, domyślne wartości dokładności i skali są odpowiednio 18 i 0. W szczególnych przypadkach obsługiwane są następujące przeciążenia `Decimal` :  
  
- `CAST( d as Edm.Decimal );`  
  
- `CAST( d as Edm.Decimal(precision) );`  
  
- `CAST( d as Edm.Decimal(precision, scale) );`  
  
 Użycie wyrażenia Cast jest uznawane za jawną konwersję. Konwersje jawne mogą obciąć dane lub utracić precyzję.  
  
> [!NOTE]
> RZUTowanie jest obsługiwane tylko dla typów pierwotnych i typów elementów członkowskich wyliczenia.  
  
## <a name="example"></a>Przykład  

 Następujące [!INCLUDE[esql](../../../../../../includes/esql-md.md)] zapytanie używa operatora Cast do rzutowania wyrażenia jednego typu danych na inny. Zapytanie jest oparte na modelu sprzedaży AdventureWorks. Aby skompilować i uruchomić to zapytanie, wykonaj następujące kroki:  
  
1. Postępuj zgodnie z procedurą w [instrukcje: wykonywanie zapytania, które zwraca wyniki typu pierwotnego](../how-to-execute-a-query-that-returns-primitivetype-results.md).  
  
2. Przekaż następujące zapytanie jako argument do `ExecutePrimitiveTypeQuery` metody:  
  
 [!code-csharp[DP EntityServices Concepts 2#CAST](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#cast)]  
  
## <a name="see-also"></a>Zobacz też

- [Odwołanie do jednostki SQL](entity-sql-reference.md)
