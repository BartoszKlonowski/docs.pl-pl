---
title: . (Dostęp do elementów członkowskich) (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 4733e3b2-3efa-4b96-b591-ac31350e96ad
ms.openlocfilehash: 82cd2f17b2b5ea484a8202b50619047b428fe94a
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91192155"
---
# <a name="-member-access-entity-sql"></a>. (Dostęp do elementów członkowskich) (Entity SQL)

Operator kropki (.) jest [!INCLUDE[esql](../../../../../../includes/esql-md.md)] operatorem dostępu elementu członkowskiego. Operator dostępu do elementu członkowskiego jest używany do uzyskania wartości właściwości lub pola wystąpienia typu modelu koncepcyjnego koncepcyjny.  
  
## <a name="syntax"></a>Składnia  
  
```sql  
expression.identifier  
```  
  
## <a name="arguments"></a>Argumenty  

 `expression`  
 Wystąpienie strukturalnego modelu koncepcyjnego.  
  
 `identifier`  
 Właściwość lub pole, które należy do wystąpienia obiektu.  
  
## <a name="remarks"></a>Uwagi  

 Operator kropki (.) może służyć do wyodrębniania pól z rekordu, podobnie jak w przypadku wyodrębniania właściwości typu złożonego lub jednostki. Na przykład jeśli n typu nazwa jest członkiem typu osoba, a p jest wystąpieniem typu Person, a p. n jest dozwolonym wyrażeniem dostępu do elementu członkowskiego, który zwraca wartość typu Name.  
  
 `select p.Name.FirstName from LOB.Person as p`  
  
## <a name="see-also"></a>Zobacz też

- [Odwołanie do jednostki SQL](entity-sql-reference.md)
