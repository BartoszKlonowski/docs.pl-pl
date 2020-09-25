---
title: 'Instrukcje: Używanie funkcji skalarnej zdefiniowanej przez użytkownika'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 714e252f-c053-4bbb-b1f3-924111cd4d97
ms.openlocfilehash: faf8d6e94c88575f6cb73003fa5bed87650d7d54
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91196939"
---
# <a name="how-to-use-scalar-valued-user-defined-functions"></a><span data-ttu-id="a5a6a-102">Instrukcje: Używanie funkcji skalarnej zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="a5a6a-102">How to: Use Scalar-Valued User-Defined Functions</span></span>

<span data-ttu-id="a5a6a-103">Można zmapować metodę klienta zdefiniowaną w klasie do funkcji zdefiniowanej przez użytkownika przy użyciu <xref:System.Data.Linq.Mapping.FunctionAttribute> atrybutu.</span><span class="sxs-lookup"><span data-stu-id="a5a6a-103">You can map a client method defined on a class to a user-defined function by using the <xref:System.Data.Linq.Mapping.FunctionAttribute> attribute.</span></span> <span data-ttu-id="a5a6a-104">Należy zauważyć, że treść metody konstruuje wyrażenie, które przechwytuje zamiar wywołania metody i przekazuje to wyrażenie do <xref:System.Data.Linq.DataContext> translacji i wykonywania.</span><span class="sxs-lookup"><span data-stu-id="a5a6a-104">Note that the body of the method constructs an expression that captures the intent of the method call, and passes that expression to the <xref:System.Data.Linq.DataContext> for translation and execution.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="a5a6a-105">Bezpośrednie wykonanie odbywa się tylko wtedy, gdy funkcja jest wywoływana poza zapytaniem.</span><span class="sxs-lookup"><span data-stu-id="a5a6a-105">Direct execution occurs only if the function is called outside a query.</span></span> <span data-ttu-id="a5a6a-106">Aby uzyskać więcej informacji, zobacz [How to: Call User-Defined Functions inline](how-to-call-user-defined-functions-inline.md).</span><span class="sxs-lookup"><span data-stu-id="a5a6a-106">For more information, see [How to: Call User-Defined Functions Inline](how-to-call-user-defined-functions-inline.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="a5a6a-107">Przykład</span><span class="sxs-lookup"><span data-stu-id="a5a6a-107">Example</span></span>  

 <span data-ttu-id="a5a6a-108">Poniższy kod SQL przedstawia funkcję skalarną zdefiniowaną przez użytkownika `ReverseCustName()` .</span><span class="sxs-lookup"><span data-stu-id="a5a6a-108">The following SQL code presents a scalar-valued user-defined function `ReverseCustName()`.</span></span>  
  
```sql  
CREATE FUNCTION ReverseCustName(@string varchar(100))  
RETURNS varchar(100)  
AS  
BEGIN  
    DECLARE @custName varchar(100)  
    -- Implementation left as exercise for users.  
    RETURN @custName  
END  
```  
  
 <span data-ttu-id="a5a6a-109">Należy zmapować metodę klienta, na przykład następujące dla tego kodu:</span><span class="sxs-lookup"><span data-stu-id="a5a6a-109">You would map a client method such as the following for this code:</span></span>  
  
 [!code-csharp[DLinqUDFS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqUDFS/cs/northwind-tfunc.cs#3)]
 [!code-vb[DLinqUDFS#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqUDFS/vb/northwind-tfunc.vb#3)]  
  
## <a name="see-also"></a><span data-ttu-id="a5a6a-110">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a5a6a-110">See also</span></span>

- [<span data-ttu-id="a5a6a-111">Funkcje zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="a5a6a-111">User-Defined Functions</span></span>](user-defined-functions.md)
