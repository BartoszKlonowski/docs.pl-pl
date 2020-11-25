---
title: StackOverflowType — Wyliczenie
ms.date: 03/30/2017
api_name:
- StackOverflowType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- StackOverflowType
helpviewer_keywords:
- StackOverflowType enumeration [.NET Framework hosting]
ms.assetid: dab648ad-972b-479c-b129-b4c1dcbd932e
topic_type:
- apiref
ms.openlocfilehash: bbdc68721378e6bbb09f5e4eade08e2e6e03b097
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95729918"
---
# <a name="stackoverflowtype-enumeration"></a><span data-ttu-id="8815f-102">StackOverflowType — Wyliczenie</span><span class="sxs-lookup"><span data-stu-id="8815f-102">StackOverflowType Enumeration</span></span>

<span data-ttu-id="8815f-103">Zawiera wartości wskazujące podstawową przyczynę zdarzenia przepełnienia stosu.</span><span class="sxs-lookup"><span data-stu-id="8815f-103">Contains values that indicate the underlying cause of a stack overflow event.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8815f-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="8815f-104">Syntax</span></span>  
  
```cpp  
typedef enum {  
    SO_Managed,  
    SO_ClrEngine,  
    SO_Other  
} StackOverflowType;  
```  
  
## <a name="members"></a><span data-ttu-id="8815f-105">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="8815f-105">Members</span></span>  
  
|<span data-ttu-id="8815f-106">Członek</span><span class="sxs-lookup"><span data-stu-id="8815f-106">Member</span></span>|<span data-ttu-id="8815f-107">Opis</span><span class="sxs-lookup"><span data-stu-id="8815f-107">Description</span></span>|  
|------------|-----------------|  
|`SO_ClrEngine`|<span data-ttu-id="8815f-108">Przepełnienie stosu zostało spowodowane przez aparat wykonywania.</span><span class="sxs-lookup"><span data-stu-id="8815f-108">The stack overflow was caused by the execution engine.</span></span>|  
|`SO_Managed`|<span data-ttu-id="8815f-109">Przepełnienie stosu zostało spowodowane przez kod zarządzany.</span><span class="sxs-lookup"><span data-stu-id="8815f-109">The stack overflow was caused by managed code.</span></span>|  
|`SO_Other`|<span data-ttu-id="8815f-110">Przepełnienie stosu zostało spowodowane przez kod niezarządzany.</span><span class="sxs-lookup"><span data-stu-id="8815f-110">The stack overflow was caused by unmanaged code.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="8815f-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="8815f-111">Remarks</span></span>  

 <span data-ttu-id="8815f-112">Te informacje są przesyłane do hosta za pomocą wywołania metody [IActionOnCLREvent:: OnEvent](iactiononclrevent-onevent-method.md) .</span><span class="sxs-lookup"><span data-stu-id="8815f-112">This information is passed to the host through a call to the [IActionOnCLREvent::OnEvent](iactiononclrevent-onevent-method.md) method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="8815f-113">Wymagania</span><span class="sxs-lookup"><span data-stu-id="8815f-113">Requirements</span></span>  

 <span data-ttu-id="8815f-114">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="8815f-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="8815f-115">**Nagłówek:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="8815f-115">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="8815f-116">**Biblioteka:** MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="8815f-116">**Library:** MSCorEE.dll</span></span>  
  
 <span data-ttu-id="8815f-117">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="8815f-117">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8815f-118">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="8815f-118">See also</span></span>

- [<span data-ttu-id="8815f-119">Hosting — Wyliczenia</span><span class="sxs-lookup"><span data-stu-id="8815f-119">Hosting Enumerations</span></span>](hosting-enumerations.md)
