---
title: MDAInfo — Struktura
ms.date: 03/30/2017
api_name:
- MDAInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- MDAInfo
helpviewer_keywords:
- MDAInfo structure [.NET Framework hosting]
ms.assetid: fb8c14f7-d461-43d1-8b47-adb6723b9b93
topic_type:
- apiref
ms.openlocfilehash: 8e88d90e3291d21888fae7aa162f84b6377658c5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95730022"
---
# <a name="mdainfo-structure"></a><span data-ttu-id="ed3fd-102">MDAInfo — Struktura</span><span class="sxs-lookup"><span data-stu-id="ed3fd-102">MDAInfo Structure</span></span>

<span data-ttu-id="ed3fd-103">Zawiera szczegółowe informacje o `Event_MDAFired` zdarzeniu, które wyzwala tworzenie zarządzanego asystenta debugowania (MDA).</span><span class="sxs-lookup"><span data-stu-id="ed3fd-103">Provides details about the `Event_MDAFired` event, which triggers the creation of a managed debugging assistant (MDA).</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ed3fd-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="ed3fd-104">Syntax</span></span>  
  
```cpp  
typedef struct _MDAInfo {  
    LPCWSTR  lpMDACaption;  
    LPCWSTR  lpMDAMessage  
} MDAInfo;  
```  
  
## <a name="members"></a><span data-ttu-id="ed3fd-105">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="ed3fd-105">Members</span></span>  
  
|<span data-ttu-id="ed3fd-106">Członek</span><span class="sxs-lookup"><span data-stu-id="ed3fd-106">Member</span></span>|<span data-ttu-id="ed3fd-107">Opis</span><span class="sxs-lookup"><span data-stu-id="ed3fd-107">Description</span></span>|  
|------------|-----------------|  
|`lpMDACaption`|<span data-ttu-id="ed3fd-108">Tytuł bieżącego elementu MDA.</span><span class="sxs-lookup"><span data-stu-id="ed3fd-108">The title of the current MDA.</span></span> <span data-ttu-id="ed3fd-109">Tytuł opisuje rodzaj błędu, który wyzwolił `Event_MDAFired` zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="ed3fd-109">The title describes the kind of failure that triggered the `Event_MDAFired` event.</span></span>|  
|`lpMDAMessage`|<span data-ttu-id="ed3fd-110">Komunikat wyjściowy dostarczony przez bieżące zdarzenie MDA.</span><span class="sxs-lookup"><span data-stu-id="ed3fd-110">The output message provided by the current MDA.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="ed3fd-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ed3fd-111">Remarks</span></span>  

 <span data-ttu-id="ed3fd-112">Zarządzane Asystenci debugowania (MDA) to pomoce debugowania, które działają w połączeniu ze środowiskiem uruchomieniowym języka wspólnego (CLR) do wykonywania zadań, takich jak identyfikowanie nieprawidłowych warunków w aparacie wykonawczym środowiska uruchomieniowego lub zatopienie dodatkowych informacji o stanie aparatu.</span><span class="sxs-lookup"><span data-stu-id="ed3fd-112">Managed debugging assistants (MDAs) are debugging aids that work in conjunction with the common language runtime (CLR) to perform tasks such as identifying invalid conditions in the runtime execution engine or dumping additional information about the state of the engine.</span></span> <span data-ttu-id="ed3fd-113">MDA generuje komunikaty XML o zdarzeniach, które w przeciwnym razie trudno jest Zalewka.</span><span class="sxs-lookup"><span data-stu-id="ed3fd-113">MDAs generate XML messages about events that are otherwise difficult to trap.</span></span> <span data-ttu-id="ed3fd-114">Są one szczególnie przydatne do debugowania przejść między zarządzanym i niezarządzanym kodem.</span><span class="sxs-lookup"><span data-stu-id="ed3fd-114">They are especially useful for debugging transitions between managed and unmanaged code.</span></span>  
  
 <span data-ttu-id="ed3fd-115">Środowisko uruchomieniowe wykonuje następujące czynności, gdy zostanie wyzwolone zdarzenie wyzwalające utworzenie elementu MDA:</span><span class="sxs-lookup"><span data-stu-id="ed3fd-115">The runtime takes the following steps when an event that triggers the creation of an MDA is fired:</span></span>  
  
- <span data-ttu-id="ed3fd-116">Jeśli host nie zarejestrował wystąpienia [IActionOnCLREvent](iactiononclrevent-interface.md) przez wywołanie [ICLROnEventManager:: RegisterActionOnEvent —](iclroneventmanager-registeractiononevent-method.md) w celu powiadomienia o `Event_MDAFired` zdarzeniu, środowisko uruchomieniowe kontynuuje działanie z domyślnym, nieobsługiwanym zachowaniem.</span><span class="sxs-lookup"><span data-stu-id="ed3fd-116">If the host has not registered an [IActionOnCLREvent](iactiononclrevent-interface.md) instance by calling [ICLROnEventManager::RegisterActionOnEvent](iclroneventmanager-registeractiononevent-method.md) to be notified of an `Event_MDAFired` event, the runtime proceeds with its default, non-hosted behavior.</span></span>  
  
- <span data-ttu-id="ed3fd-117">Jeśli host zarejestrował procedurę obsługi dla tego zdarzenia, środowisko uruchomieniowe sprawdzi, czy debuger jest dołączony do procesu.</span><span class="sxs-lookup"><span data-stu-id="ed3fd-117">If the host has registered a handler for this event, the runtime checks to see whether a debugger is attached to the process.</span></span> <span data-ttu-id="ed3fd-118">Jeśli tak jest, środowisko uruchomieniowe jest przerywane w debugerze.</span><span class="sxs-lookup"><span data-stu-id="ed3fd-118">If it is, the runtime breaks into the debugger.</span></span> <span data-ttu-id="ed3fd-119">Gdy debuger kontynuuje działanie, wywołuje hosta.</span><span class="sxs-lookup"><span data-stu-id="ed3fd-119">When the debugger continues, it calls into the host.</span></span> <span data-ttu-id="ed3fd-120">Jeśli debuger nie jest dołączony, środowisko uruchomieniowe wywołuje `IActionOnCLREvent::OnEvent` i przekazuje wskaźnik do `MDAInfo` wystąpienia jako `data` parametr.</span><span class="sxs-lookup"><span data-stu-id="ed3fd-120">If no debugger is attached, the runtime calls `IActionOnCLREvent::OnEvent` and passes a pointer to an `MDAInfo` instance as the `data` parameter.</span></span>  
  
 <span data-ttu-id="ed3fd-121">Host może zdecydować się na aktywację MDA i otrzymywanie powiadomień, gdy zostanie uaktywnione zdarzenie MDA.</span><span class="sxs-lookup"><span data-stu-id="ed3fd-121">The host can choose to activate MDAs and to be notified when an MDA is activated.</span></span> <span data-ttu-id="ed3fd-122">Dzięki temu host może przesłonić domyślne zachowanie i przerwać zarządzany wątek, który wywołał zdarzenie, aby zapobiec uszkodzeniu stanu procesu.</span><span class="sxs-lookup"><span data-stu-id="ed3fd-122">This gives the host an opportunity to override default behavior and to abort the managed thread that raised the event, to prevent it from corrupting the process state.</span></span> <span data-ttu-id="ed3fd-123">Aby uzyskać więcej informacji na temat korzystania z programu MDA, zobacz [Diagnozowanie błędów przy użyciu asystentów zarządzanego debugowania](../../debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md).</span><span class="sxs-lookup"><span data-stu-id="ed3fd-123">For more information about using MDAs, see [Diagnosing Errors with Managed Debugging Assistants](../../debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md).</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ed3fd-124">Wymagania</span><span class="sxs-lookup"><span data-stu-id="ed3fd-124">Requirements</span></span>  

 <span data-ttu-id="ed3fd-125">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="ed3fd-125">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ed3fd-126">**Nagłówek:** MSCorEE. idl</span><span class="sxs-lookup"><span data-stu-id="ed3fd-126">**Header:** MSCorEE.idl</span></span>  
  
 <span data-ttu-id="ed3fd-127">**Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="ed3fd-127">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="ed3fd-128">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="ed3fd-128">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ed3fd-129">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="ed3fd-129">See also</span></span>

- [<span data-ttu-id="ed3fd-130">Hosting — Struktury</span><span class="sxs-lookup"><span data-stu-id="ed3fd-130">Hosting Structures</span></span>](hosting-structures.md)
- [<span data-ttu-id="ed3fd-131">Diagnozowanie błędów przy użyciu asystentów zarządzanego debugowania</span><span class="sxs-lookup"><span data-stu-id="ed3fd-131">Diagnosing Errors with Managed Debugging Assistants</span></span>](../../debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
