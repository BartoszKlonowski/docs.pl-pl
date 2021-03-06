---
title: WIERSZ (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 06da96e8-55d7-486c-991a-4e514d837ff9
ms.openlocfilehash: 2ab91d0c6d3c3ed3f88a7f0ddbf3a6c2f36d8b04
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91202256"
---
# <a name="row-entity-sql"></a>WIERSZ (Entity SQL)

Konstruuje anonimowe, strukturalnie wpisane rekordy z co najmniej jednej wartości.  
  
## <a name="syntax"></a>Składnia  
  
```sql  
ROW ( expression [ AS alias ] [,...] )  
```  
  
## <a name="arguments"></a>Argumenty  

 `expression`  
 Każde prawidłowe wyrażenie zapytania, które zwraca wartość do skonstruowania w typie wiersza.  
  
 `alias`  
 Określa alias dla wartości określonej w typie wiersza. Jeśli nie podano aliasu, program [!INCLUDE[esql](../../../../../../includes/esql-md.md)] podejmie próbę wygenerowania aliasu na podstawie [!INCLUDE[esql](../../../../../../includes/esql-md.md)] reguł generowania aliasów.  
  
## <a name="return-value"></a>Wartość zwracana  

 Typ wiersza.  
  
## <a name="remarks"></a>Uwagi  

 Konstruktory wierszy w programie służą [!INCLUDE[esql](../../../../../../includes/esql-md.md)] do konstruowania anonimowych, strukturalnie wpisanych rekordów z co najmniej jednej wartości. Typ wyniku konstruktora wierszy jest typem wiersza, którego typy pól odpowiadają typom wartości, które były używane do konstruowania wiersza. Na przykład następujące wyrażenie konstruuje wartość typu `Record(a int, b string, c int)` .  
  
```sql  
ROW(1 AS a, "abc" AS b, a+34 AS c)  
```  
  
 Jeśli nie podasz aliasu dla wyrażenia w konstruktorze wierszy, Entity Framework podejmie próbę wygenerowania jednego. Aby uzyskać więcej informacji, zobacz sekcję "reguły aliasów" tematu [identyfikatory](identifiers-entity-sql.md) .  
  
 W konstruktorze wierszy są stosowane następujące reguły:  
  
- Wyrażenia w konstruktorze wierszy nie mogą odwoływać się do innych aliasów w tym samym konstruktorze.  
  
- Dwa wyrażenia w tym samym konstruktorze wierszy nie mogą mieć tego samego aliasu.  
  
 Aby uzyskać więcej informacji na temat konstruktorów zapytań, zobacz [konstruowanie typów](constructing-types-entity-sql.md).  
  
## <a name="example"></a>Przykład  

 Poniższe zapytanie Entity SQL używa operatora wiersza do konstruowania anonimowych, strukturalnych rekordów z określonym typem. Zapytanie jest oparte na modelu sprzedaży AdventureWorks. Aby skompilować i uruchomić to zapytanie, wykonaj następujące kroki:  
  
1. Postępuj zgodnie z procedurą w temacie [How to: Execute a Query zwracającej wyniki StructuralType](../how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2. Przekaż następujące zapytanie jako argument do `ExecuteStructuralTypeQuery` metody:  
  
 [!code-sql[DP EntityServices Concepts#ROW](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#row)]  
  
## <a name="see-also"></a>Zobacz też

- [Konstruowanie typów](constructing-types-entity-sql.md)
- [Odwołanie do jednostki SQL](entity-sql-reference.md)
- [Definicje typu](type-definitions-entity-sql.md)
