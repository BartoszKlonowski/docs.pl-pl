---
title: 'Dostosowywanie operacji: Omówienie'
ms.date: 03/30/2017
ms.assetid: a3546296-1443-4b88-aa6e-d41011041ba7
ms.openlocfilehash: d4d375716e3199afcbbb9bbd8b8b04867ca0e5fa
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91173526"
---
# <a name="customizing-operations-overview"></a><span data-ttu-id="6f3b9-102">Dostosowywanie operacji: Omówienie</span><span class="sxs-lookup"><span data-stu-id="6f3b9-102">Customizing Operations: Overview</span></span>

<span data-ttu-id="6f3b9-103">Domyślnie program [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] generuje dynamiczny SQL dla operacji INSERT, Update i DELETE na podstawie mapowania.</span><span class="sxs-lookup"><span data-stu-id="6f3b9-103">By default, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] generates dynamic SQL for insert, update, and delete operations based on mapping.</span></span> <span data-ttu-id="6f3b9-104">Jednak w przypadku zwykle warto dodać własną logikę biznesową, aby zapewnić bezpieczeństwo, sprawdzanie poprawności i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="6f3b9-104">However, in practice you typically want to add your own business logic to provide for security, validation, and so forth.</span></span>  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="6f3b9-105">metody dostosowywania tych operacji obejmują następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6f3b9-105">techniques for customizing these operations include the following.</span></span>  
  
## <a name="loading-options"></a><span data-ttu-id="6f3b9-106">Opcje ładowania</span><span class="sxs-lookup"><span data-stu-id="6f3b9-106">Loading Options</span></span>  

 <span data-ttu-id="6f3b9-107">W zapytaniach można kontrolować, ile danych związanych z głównym celem jest pobieranych podczas łączenia się z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="6f3b9-107">In your queries, you can control how much data related to your main target is retrieved when you connect to the database.</span></span> <span data-ttu-id="6f3b9-108">Ta funkcja jest wdrażana za pomocą programu <xref:System.Data.Linq.DataLoadOptions> .</span><span class="sxs-lookup"><span data-stu-id="6f3b9-108">This functionality is implemented largely by using <xref:System.Data.Linq.DataLoadOptions>.</span></span> <span data-ttu-id="6f3b9-109">Aby uzyskać więcej informacji, zobacz [odroczone względem natychmiastowego ładowania](deferred-versus-immediate-loading.md).</span><span class="sxs-lookup"><span data-stu-id="6f3b9-109">For more information, see [Deferred versus Immediate Loading](deferred-versus-immediate-loading.md).</span></span>  
  
## <a name="partial-methods"></a><span data-ttu-id="6f3b9-110">Metody częściowe</span><span class="sxs-lookup"><span data-stu-id="6f3b9-110">Partial Methods</span></span>  

 <span data-ttu-id="6f3b9-111">W domyślnym mapowaniu program [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] udostępnia metody częściowe, które ułatwiają wdrożenie logiki biznesowej.</span><span class="sxs-lookup"><span data-stu-id="6f3b9-111">In its default mapping, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] provides partial methods to help you implement your business logic.</span></span> <span data-ttu-id="6f3b9-112">Aby uzyskać więcej informacji, zobacz [Dodawanie logiki biznesowej przy użyciu metod częściowych](adding-business-logic-by-using-partial-methods.md).</span><span class="sxs-lookup"><span data-stu-id="6f3b9-112">For more information, see [Adding Business Logic By Using Partial Methods](adding-business-logic-by-using-partial-methods.md).</span></span>  
  
## <a name="stored-procedures-and-user-defined-functions"></a><span data-ttu-id="6f3b9-113">Procedury składowane i funkcje zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="6f3b9-113">Stored Procedures and User-Defined Functions</span></span>  

 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="6f3b9-114">obsługuje korzystanie z procedur składowanych i funkcji zdefiniowanych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6f3b9-114">supports the use of stored procedures and user-defined functions.</span></span> <span data-ttu-id="6f3b9-115">Procedury składowane są często używane do dostosowywania operacji.</span><span class="sxs-lookup"><span data-stu-id="6f3b9-115">Stored procedures are frequently used to customize operations.</span></span> <span data-ttu-id="6f3b9-116">Aby uzyskać więcej informacji, zobacz [procedury składowane](stored-procedures.md).</span><span class="sxs-lookup"><span data-stu-id="6f3b9-116">For more information, see [Stored Procedures](stored-procedures.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6f3b9-117">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6f3b9-117">See also</span></span>

- [<span data-ttu-id="6f3b9-118">Dostosowywanie operacji wstawiania, aktualizowania i usuwania</span><span class="sxs-lookup"><span data-stu-id="6f3b9-118">Customizing Insert, Update, and Delete Operations</span></span>](customizing-insert-update-and-delete-operations.md)
